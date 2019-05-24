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

end