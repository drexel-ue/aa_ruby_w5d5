## Monkey Patching
### my_flatten

Write a method that flattens an array to the specified level. If no level
is specified, it should entirely flatten nested arrays.

Examples:

```ruby
# Without an argument:
[["a"], "b", ["c", "d", ["e"]]].my_flatten = ["a", "b", "c", "d", "e"]

# When given 1 as an argument:
# (Flattens the first level of nested arrays but no deeper)
[["a"], "b", ["c", "d", ["e"]]].my_flatten(1) = ["a", "b", "c", "d", ["e"]]





### Merge Sort

Write a new `Array#merge_sort` method that takes in a proc; it should not modify the array it is called on, but create a new sorted array.

class Array

    def self.merge(left, right, &prc)

        merged_arr = []

        until left.empty? || right.empty?
            case prc.call(left, right)
                when -1
                    merged_arr << left.shift
                when 0
                    merged_arr << left.shift
                when 1
                    merged_arr << right.shift
            end
        end

        merged_arr + left + right

    end

    def merge_sort(&prc)
        prc ||= Proc.new { |a, b| a <=> b }

        midpoint = self.length / 2
        left = self.take(midpoint)
        right = self.drop(midpoint)

        Array.merge(left.merg_sort(prc) right.merg_sort(prc), prc)

    end

    def my_flatten(level = nil)
        return [self[0]] if length == 1 && !self[0].is_a?(Array)

        flattened = []
        
        if !level.nil?
            while level > 0
                (0...length).each do |index|
                    if self[index].is_a?(Array)
                        flattened << self[index].my_flatten(level - 1)
                    else
                        flattened << self[i]
                    end
                end

            end
        else
            until !self.any? { |el| el.is_a?(Array) }
                (0...length).each do |index|
                    if self[index].is_a?(Array)
                        flattened << self[index].my_flatten(level - 1)
                    else
                        flattened << self[i]
                    end
                end
            end
        end

        flattened
    end



end